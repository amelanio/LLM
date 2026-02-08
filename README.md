# ProPaHer - Sistema RAG de Búsqueda Semántica de Precios

## El Problema y La Solución

Las empresas de construcción gestionan miles de presupuestos históricos en archivos Excel dispersos, lo que genera búsquedas manuales de 2-3 horas por partida, inconsistencia de precios, y variaciones idiomáticas (catalán/castellano) imposibles de encontrar. ProPaHer implementa un sistema RAG (Retrieval-Augmented Generation) que centraliza, normaliza e indexa toda la información mediante embeddings semánticos de 384 dimensiones, permitiendo búsquedas por similitud de significado en <1 segundo con 95-99% de precisión. El sistema calcula automáticamente estadísticas de precio (media, mediana, ponderada) y encuentra todas las variantes de un concepto sin importar cómo esté escrito.

## Arquitectura y Tecnologías

El sistema se compone de 5 notebooks Jupyter que implementan el pipeline completo: **Notebook 1** (Preparación) usa pandas y openpyxl para extraer y normalizar partidas de Excel; **Notebook 2** (Indexación) emplea ChromaDB y Sentence Transformers (modelo paraphrase-multilingual-MiniLM-L12-v2) para generar embeddings y crear una base de datos vectorial con búsqueda HNSW; **Notebook 3** (Búsqueda Técnica) proporciona análisis avanzado con matplotlib para desarrolladores; **Notebook 4** (API Testing) valida la API REST construida con FastAPI; y **Notebook 5** (Interfaz Gradio) ofrece una interfaz web visual en localhost:7860 para usuarios finales sin conocimientos técnicos. El stack incluye Python 3.11, ChromaDB, FastAPI, Gradio, y permite integraciones con n8n y Telegram Bot.

## Escalabilidad: 2000 Presupuestos Históricos

El sistema está diseñado para escalar de un piloto con 50 presupuestos hasta implementaciones empresariales con 2000+ presupuestos y ~300,000 partidas. El procesamiento de 2000 Excel toma 2-4 horas (Notebook 1), la generación de embeddings e indexación requiere 3-6 horas en CPU o 30-60 minutos con GPU (Notebook 2), resultando en una base de datos de 10-15GB que mantiene tiempos de búsqueda de 50-200ms. La estrategia de implementación incluye 5 fases: piloto (1 semana), procesamiento batch (1-2 días), indexación (medio día), validación (1-2 días) y producción (1 día). Las optimizaciones recomendadas incluyen procesamiento paralelo con multiprocessing, uso de GPU para embeddings (10-20x más rápido), indexación incremental para nuevos datos, y caché Redis para búsquedas frecuentes.

## Roadmap de Mejoras Futuras

 Generación automática de presupuestos mediante IA generativa describiendo proyectos en lenguaje natural, integración con BIM para extraer cantidades de modelos IFC, marketplace colaborativo de precios entre empresas, análisis predictivo avanzado para optimización de licitaciones, y multimodalidad con OCR de presupuestos escaneados, procesamiento de voz y reconocimiento de planos mediante visión computacional.

## Beneficios Medibles e Impacto

El sistema reduce el tiempo de búsqueda de 1-3 horas a <5 segundos, generando un ahorro estimado de 400 horas/mes por empresa. La precisión aumenta de 40-60% (búsqueda manual) a 95-99% (búsqueda semántica), con detección automática del 100% de variaciones idiomáticas. Los beneficios de negocio incluyen presupuestos más precisos con reducción de desviaciones, respuesta más rápida a clientes (presupuestos en horas vs días), conocimiento centralizado disponible 24/7 sin depender de memoria humana, y decisiones basadas en análisis histórico robusto con identificación de tendencias. El ROI se materializa en mayor competitividad, mejor estimación de costes, y eliminación de tiempo perdido en búsquedas manuales.
