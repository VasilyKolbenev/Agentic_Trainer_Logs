# ESK Agentic Bot — PRO (LLM-only, few-shot, buttons, HITL)

Функционал:
- Few-shot классификация доменов — LLM (batched), без эвристик.
- Обработка .xlsx → нормализация → авторазметка → HITL-очередь на «сомнительные» → LLM-аугментация → dataset train/eval.
- Инлайн-кнопки: главное меню, top‑3 домена для быстрой коррекции, управление очередью ревью, экспорт.
- **🧠 Система активного обучения** — запоминает исправления и улучшает точность.
- **💾 Кэширование LLM** — экономия токенов на повторяющихся запросах.
- **📊 Прогресс-бары** — визуальный прогресс обработки больших файлов.
- **👤 Персональные контексты** — адаптация под каждого пользователя.
- **📈 Расширенная аналитика** — детальная статистика качества и использования.

## 🚀 Быстрый старт

### Локальная установка
```bash
# 1. Клонируем репозиторий
git clone https://github.com/your-username/esk-agent-llm-pro.git
cd esk-agent-llm-pro

# 2. Создаем виртуальное окружение  
python -m venv .venv
# Windows:
.venv\Scripts\activate
# Linux/Mac:
source .venv/bin/activate

# 3. Устанавливаем зависимости
pip install -r requirements.txt

# 4. Настраиваем конфигурацию
cp config.example .env
# Отредактируйте .env: укажите TELEGRAM_BOT_TOKEN и LLM_API_KEY

# 5. Проверяем систему
python health_check.py

# 6. Запускаем бота
python -m src.bot
```

## ☁️ Railway Deploy
- Deploy from GitHub
- Variables: BOT_TOKEN, LLM_API_KEY, (LLM_API_BASE), (PUBLIC_URL)  
- Start Command: `python -m src.bot`

## 🏠 Локальные LLM модели
Система поддерживает подключение локальных моделей через OpenAI-совместимые API:

```bash
# Ollama
LLM_API_BASE=http://localhost:11434/v1
LLM_MODEL=llama3.1:8b

# vLLM
LLM_API_BASE=http://localhost:8000/v1  
LLM_MODEL=microsoft/DialoGPT-large

# LM Studio
LLM_API_BASE=http://localhost:1234/v1
LLM_MODEL=local-model
```

Подробнее в `ARCHITECTURE.md`.

## Команды
- `/menu` — главное меню с кнопками
- `/start`, `/help` — помощь
- `/stats` — **детальная аналитика системы**
- Загрузить .xlsx/.csv — автообработка с прогресс-баром
- Кнопки top‑3 — быстрое исправление классификации (система запоминает!)
- «Очередь ревью» — пошаговая разметка низкой уверенности
- «Экспорт датасета» — отправка `dataset_train.jsonl` и `dataset_eval.jsonl`

## 🔧 Проверка системы
```bash
python health_check.py  # Проверить готовность к работе
```

## 📖 Документация
- `USAGE_GUIDE.md` — подробное руководство пользователя
- `config.example` — пример конфигурации

Порог `LOW_CONF`, батч `BATCH_SIZE`, параллелизм `RATE_LIMIT` — через .env.
