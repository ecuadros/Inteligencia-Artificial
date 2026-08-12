# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Interactive web application for a university-level Introduction to Artificial Intelligence course (Engineering track). Each module contains visual, hands-on demos showing AI concepts running live in the browser, tied to real engineering problems. Sister project to [Algebra-y-Geometria](https://github.com/ecuadros/Algebra-y-Geometria) — same visual language, same interaction model, same author.

Deployed as a static site via **GitHub Pages** (Jekyll). No backend. All computation — including neural network training and inference — runs client-side in the browser.

## Tech Stack

- **Jekyll** — static site generator (GitHub Pages compatible)
- **TensorFlow.js** — live neural network training/inference in the browser (perceptron, MLP, CNN demos)
- **D3.js** — 2D charts, decision boundaries, embeddings, attention maps
- **Three.js** — 3D visualizations where useful (loss landscapes, search spaces)
- **Vanilla JS / Canvas 2D** — lightweight interactive demos (grids, games, drawing pads)

## Planned Module Structure

Each module lives in its own directory with self-contained HTML pages and JS logic. The final project is a standalone top-level section (not a module), same pattern as `Examenes/` in Algebra-y-Geometria.

```
/modulo-01-agentes/
/modulo-02-busqueda-juegos/
/modulo-03-aprendizaje-supervisado/
/modulo-04-no-supervisado-refuerzo/
/modulo-05-redes-neuronales/
/modulo-06-vision-computadora/
/modulo-07-nlp/
/modulo-08-etica-generativa/
/proyecto-final/
_layouts/
_includes/
assets/
  js/
  css/
```

Each demo page should be independently usable (no shared state between pages). Shared utilities (TF.js model helpers, canvas drawing primitives, D3 chart helpers) go in `assets/js/`.

## Modules and Demos (16 weeks)

| # | Módulo | Semanas | Demos interactivos | Puente con Álgebra y Geometría |
|---|--------|---------|---------------------|----------------------------------|
| 1 | Agentes Inteligentes | 1 | Test de Turing jugable · Robot aspiradora reactivo en grid · Diseñador de PEAS | — |
| 2 | Búsqueda y Juegos | 2–3 | Pathfinding BFS/DFS/A* en laberinto · Minimax + poda alfa-beta en tres-en-línea · Hill climbing sobre paisaje 3D | Módulo 6 (superficies, parametrización) |
| 3 | Aprendizaje Supervisado | 4–5 | Regresión lineal con descenso de gradiente animado · Frontera de decisión manipulable (logística/SVM) · Árbol de decisión visual | Módulo 3 (mínimos cuadrados, pseudoinversa) |
| 4 | No Supervisado y por Refuerzo | 6–7 | K-means paso a paso · Segmentación de clientes · Q-learning jugable en grid world | Módulo 5 (PCA, reducción de dimensionalidad) |
| 5 | Redes Neuronales y Deep Learning | 8–9 | Perceptrón con pesos ajustables a mano · Red TF.js entrenando en vivo sobre dígitos dibujados · Visualizador de retropropagación | Módulo 2 (transformaciones, composición) |
| 6 | Visión por Computadora | 10–11 | Filtros de convolución sobre imagen/cámara en vivo · Reconocedor de dígitos dibujados (TF.js) · Mapa de feature maps de una CNN | Módulo 2 (convolución de imágenes — mismo demo, otra lectura) |
| 7 | Procesamiento de Lenguaje Natural | 12–13 | Visualizador de embeddings 2D/3D (word2vec) · Mapa de atención de un mini-transformer · Chatbot simple con LLM API | Módulo 1 (similitud coseno — mismo demo, reutilizable) |
| 8 | Ética y IA Generativa | 14 | Demo de sesgo algorítmico en un dataset real · Cómo funciona un modelo de difusión (simplificado) | — |
| — | Proyecto Final | 15–16 | Sección independiente (no módulo): rúbrica, entregables, presentación en vivo | — |

## Development

Since this is a Jekyll site served via GitHub Pages, local development uses:

```bash
bundle install          # first time only
bundle exec jekyll serve --livereload
# Site runs at http://localhost:4000
```

To add a new demo page, create a file with Jekyll front matter:

```yaml
---
layout: demo
title: "Título del Demo"
module: 5
---
```

## Design Principles

- Each demo must work without any server calls — all data and computation is local, including model training (TensorFlow.js runs entirely client-side via WebGL).
- Demos should be parametric: sliders, drag handles, drawing pads, and inputs that let students manipulate values and see results instantly — no static screenshots standing in for interactivity.
- Every demo page ties the concept back to a concrete engineering problem before showing the math/algorithm, same narrative structure as Algebra-y-Geometria.
- Mobile-friendly is a nice-to-have, but desktop-first is acceptable given the course context.
- Spanish is the primary language for UI text (course is taught in Spanish).
