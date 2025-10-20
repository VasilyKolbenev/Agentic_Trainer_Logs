# 📦 Установка зависимостей

## ⚡ Быстрая установка

```bash
pip install -r requirements.txt
```

**Важно:** PydanticAI может требовать Python 3.10+

---

## 🔧 Пошаговая установка

### 1. Проверка Python версии

```bash
python --version
# Должно быть: Python 3.10 или выше
```

Если версия ниже - обновите Python.

---

### 2. Создание виртуального окружения (рекомендуется)

```bash
# Создание
python -m venv .venv

# Активация (Windows)
.venv\Scripts\activate

# Активация (Linux/Mac)
source .venv/bin/activate
```

---

### 3. Обновление pip

```bash
python -m pip install --upgrade pip
```

---

### 4. Установка зависимостей

```bash
pip install -r requirements.txt
```

Если ошибка с `pydantic-ai`:

```bash
# Установите вручную
pip install pydantic-ai

# Или используйте --no-deps если конфликты
pip install --no-deps pydantic-ai
pip install -r requirements.txt
```

---

## ⚠️ Если PydanticAI не устанавливается

### Вариант A: Установка из исходников

```bash
pip install git+https://github.com/pydantic/pydantic-ai.git
```

### Вариант B: Работа без PydanticAI (fallback)

Если PydanticAI недоступна, код автоматически использует чистый OpenAI API через обертки совместимости в `src/labeler.py` и `src/augmenter.py`.

**Ничего менять не нужно!** Просто уберите импорт:

```python
# В requirements.txt закомментируйте:
# pydantic-ai>=0.0.14
```

Проект будет работать через старые модули с теми же функциями.

---

## 🧪 Проверка установки

```bash
# Проверка всех зависимостей
python -c "import fastapi; print('FastAPI:', fastapi.__version__)"
python -c "import pydantic; print('Pydantic:', pydantic.__version__)"
python -c "import pandas; print('Pandas:', pandas.__version__)"
python -c "import sklearn; print('sklearn: OK')"

# Проверка PydanticAI (опционально)
python -c "import pydantic_ai; print('PydanticAI:', pydantic_ai.__version__)"
```

---

## 🚀 После установки

### Проверка работоспособности:

```bash
# Запуск тестов
python test_pipeline.py

# Должно вывести:
# ✅ Все импорты успешны
# ✅ Конфигурация загружена
# ...
```

---

## 📋 Troubleshooting

### Ошибка: `No module named 'pydantic_ai'`

**Решение 1:**
```bash
pip install pydantic-ai
```

**Решение 2 (если не работает):**
```bash
# Используйте Docker - там всё уже установлено
docker-compose up -d
```

**Решение 3 (fallback):**
Закомментируйте в `requirements.txt`:
```txt
# pydantic-ai>=0.0.14
```

Проект будет работать через обертки совместимости.

---

### Ошибка: `Microsoft Visual C++ required`

На Windows может требоваться компилятор для некоторых пакетов:

```bash
# Установите Build Tools:
# https://visualstudio.microsoft.com/visual-cpp-build-tools/

# Или используйте готовые wheels:
pip install --only-binary :all: -r requirements.txt
```

---

### Ошибка: конфликты версий

```bash
# Чистая установка
pip install --upgrade --force-reinstall -r requirements.txt
```

---

## ✅ Готово к запуску

После успешной установки:

```bash
# Локально
python -m uvicorn src.api:app --reload

# Или Docker (проще)
docker-compose up -d
```

**API доступен:** http://localhost:8000/docs

---

## 💡 Рекомендация

**Используйте Docker** - там всё уже настроено и работает из коробки:

```bash
docker-compose up -d
```

Не нужно ничего устанавливать локально! 🐳

