# Science Helpy 3.0

> **STATUS: ALPHA / PRE-MVP**
> Самая ранняя альфа. Функционал урезан, баги возможны — проект в стадии активного экспериментирования.

**Science Helpy 3.0** — мультиагентная система на Python + LangGraph для работы с научными статьями (arXiv). Помогает быстро находить, оценивать и разбирать публикации.

![Graph Architecture](graph_mas_2026-03-11.png)
*(Граф выполнения агентов)*

## Как это работает

Три специализированных агента, которые работают в связке:

**Coordinator Agent** — основной "мозг". Принимает запрос на естественном языке, ищет статьи через arXiv API, скачивает PDF, парсит текст и распределяет задачи между остальными агентами. Инструменты: arXiv API, PyMuPDF, Tavily Search.

**Eval Agent** — рецензент. Оценивает статью по критериям ведущих конференций (ACL, NeurIPS): новизна, методология, влияние. Выдаёт вердикт Accept/Reject с развёрнутым обоснованием.

**Writer Agent** — пишет структурированный обзор на русском. Выделяет ключевые инсайты, результаты экспериментов и практическую пользу. При необходимости гуглит незнакомые термины.

## Стек

- Python 3.11+
- LangGraph + LangChain — оркестрация агентов
- OpenRouter (DeepSeek, Llama 3, Qwen и др.) или OpenAI
- arXiv API — поиск и метаданные
- PyMuPDF4LLM — парсинг PDF в Markdown
- Pydantic — валидация и структурированный вывод

## Установка

```bash
git clone https://github.com/your-username/science-helpy-3.git
cd science-helpy-3
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Создайте `.env` в корне:

```env
OPENROUTER_API_KEY=your_openrouter_key
OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
TAVILY_API_KEY=your_tavily_key
```

## Запуск

```bash
python science_helpy_3/graph_mas.py
```

Примеры запросов:
- "Найди последние статьи про Qwen3"
- "Скачай технический отчет Qwen3 и оцени его"
- "Напиши подробный обзор на эту статью"

## Структура

```
science_helpy_3/
├── agents/
│   ├── coordinator_agent.py
│   ├── review_agent.py
│   └── writer_agent.py
├── agent_tools/
│   └── tools.py
├── downloads/
└── graph_mas.py
```

## Лицензия

MIT
