# 🛡️ Compliance Checker для 230-ФЗ
**AI-powered инструмент для автоматической проверки текстов коллекторов на соответствие российскому законодательству.**

Разработан [Антоненко Сергей] | AI Solutions Architect / Product Owner

---

## 💼 Business Value (Бизнес-ценность)
Этот проект решает проблему **рисков и штрафов** в финтехе и взыскании долгов.

| Проблема | Решение | Результат |
|----------|---------|-----------|
| Человеческий фактор при проверке скриптов | AI-валидация за 2 секунды | Снижение риска штрафов ФССП |
| Утечка данных в облачные LLM | **Local-First RAG** (ChromaDB) | Полное соответствие 152-ФЗ |
| Нестабильность внешних API | Гибридная архитектура (LLM + Fallback) | SLA > 99% доступности |

---

## 🏗 Архитектура
Система построена по принципу **RAG (Retrieval-Augmented Generation)** с локальным векторным поиском.

```mermaid
graph LR
    A[Входящий текст СМС/скрипта] --> B(Embedding Model)
    B --> C[(ChromaDB Vector Store)]
    C --> D{Semantic Search}
    D --> E[Prompt Builder + Context Injection]
    E --> F[LLM / Rule Engine Fallback]
    F --> G[JSON Response: Violations + Articles]
---

🛠 Технологический стек
Язык: Python 3.10+
Векторная БД: ChromaDB (Persistent Local Storage)
Эмбеддинги: paraphrase-multilingual-MiniLM-L12-v2 (CPU-optimized)
Валидация: Pydantic (Schema-driven output)
LLM Router: OpenRouter (Multi-provider fallback logic)
Среда: Google Colab (4GB RAM optimized)
🚀 Особенности реализации (Senior Level)
Contract-Driven Design: Жесткая JSON-схема ответа для безопасной интеграции с CRM.
Semantic Gap Bridge: Обогащение индекса синонимами (юридический термин vs разговорный язык).
Resilience: Автоматическое переключение на Rule-based логику при недоступности LLM.
Data Privacy: Текст закона и векторная база хранятся локально, данные не покидают контур.
📂 Структура проекта
├── notebooks/
│   ├── 01_mvp_compliance_checker.ipynb   (Архитектура и Mock-режим)
│   ├── 02_rag_implementation.ipynb       (Векторная БД и индексация)
│   └── 03_final_rag_pipeline.ipynb       (Полный пайплайн + Fallback)
├── assets/                               (Скриншоты и диаграммы)
└── README.md
---

🏁 Как запустить
Откройте любой ноутбук из папки notebooks/ в Google Colab.
Запустите ячейки последовательно (Runtime -> Run all).
Для работы с реальным LLM добавьте ключ в переменную API_KEY (необязательно, есть режим симуляции)
