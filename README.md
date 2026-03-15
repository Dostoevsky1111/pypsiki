
```markdown
# 🛸 Alien Signal Classifier

> **МПОШ. Продуктовый сектор. Раздел "ИТ". Практика заключительного этапа.**

Приложение для классификации радиосигналов инопланетных цивилизаций с помощью нейронной сети. Разработано в рамках олимпиады МПОШ 2026.

---

## 📋 Оглавление

- [О проекте](#-о-проекте)
- [Функциональные возможности](#-функциональные-возможности)
- [Технологический стек](#-технологический-стек)
- [Структура проекта](#-структура-проекта)
- [Установка и запуск](#-установка-и-запуск)
- [Использование](#-использование)
- [API](#-api)
- [Тестирование](#-тестирование)
- [Развёртывание в Yandex DataSphere](#-развёртывание-в-yandex-datasphere)
- [Вклад в проект](#-вклад-в-проект)
- [Лицензия](#-лицензия)

---

## 🔍 О проекте

В 2226 году Земля установила контакт с множеством инопланетных цивилизаций. Данный проект помогает учёному Михаилу автоматически определять цивилизацию-отправителя по записи радиосигнала.

**Основные задачи:**
1. 🔧 Восстановление повреждённых обозначений классов в обучающей выборке
2. 🧠 Обучение нейронной сети для классификации сигналов (запрещено использование готовых моделей)
3. 🖥️ Разработка веб-приложения с графическим интерфейсом и авторизацией
4. 📊 Визуализация аналитики и метрик качества модели

---

## ✨ Функциональные возможности

### 👤 Роли пользователей

| Роль | Возможности |
|------|-------------|
| **Администратор** | Создание новых пользователей (Имя, Фамилия, логин, пароль) |
| **Пользователь** | Загрузка тестовых данных, просмотр аналитики, получение прогнозов |

### 📈 Аналитика в интерфейсе пользователя

- 📉 График зависимости точности на валидации от количества эпох обучения
- 🥧 Диаграмма распределения записей по классам в обучающей выборке
- 🎯 Диаграмма точности классификации для каждой записи тестового набора
- 🔝 Топ-5 наиболее часто встречающихся классов в валидационной выборке
- 📊 Отображение метрик `accuracy` и `loss` на тестовых данных

### 🔐 Безопасность

- Хэширование паролей с использованием `salt` + `MD5/SHA-256`
- Сессии пользователей с таймаутом
- Валидация загружаемых файлов (формат `.npz`)

---

## 🛠 Технологический стек

```
🧠 ML / Data Science
├── Python 3.10+
├── TensorFlow / Keras — построение и обучение нейросети
├── NumPy — работа с массивами и .npz-файлами
├── Librosa / SciPy — обработка WAV-сигналов
├── Matplotlib / Plotly — визуализация графиков

🌐 Backend
├── Flask — веб-фреймворк
├── SQLAlchemy — ORM для работы с БД
├── Flask-Login — управление сессиями пользователей

🗄️ База данных
├── SQLite (для локальной разработки) / PostgreSQL (для продакшена)

🎨 Frontend
├── HTML5 / CSS3 / JavaScript
├── Bootstrap 5 — адаптивный интерфейс
├── Chart.js — интерактивные диаграммы

🧪 Тестирование и инструменты
├── pytest — unit-тесты
├── Git — система контроля версий
├── Yandex DataSphere — облачная платформа для обучения моделей
```

---

## 📁 Структура проекта

```
alien-classifier/
├── app/
│   ├── __init__.py          # Инициализация Flask-приложения
│   ├── models/
│   │   ├── user.py          # Модель пользователя
│   │   └── signal_net.py    # Архитектура нейросети
│   ├── routes/
│   │   ├── auth.py          # Маршруты авторизации
│   │   ├── admin.py         # Маршруты администратора
│   │   ├── user.py          # Маршруты пользователя
│   │   └── api.py           # REST API endpoints
│   ├── templates/           # HTML-шаблоны (Jinja2)
│   ├── static/
│   │   ├── css/             # Стили
│   │   ├── js/              # Скрипты (Chart.js, загрузка файлов)
│   │   └── uploads/         # Временное хранение загруженных файлов
│   └── utils/
│       ├── data_loader.py   # Загрузка и предобработка .npz
│       ├── decoder.py       # Восстановление классов (маппинг строк → int)
│       └── metrics.py       # Расчёт и визуализация метрик
├── data/
│   ├── raw/                 # Исходные данные (не в Git)
│   ├── processed/           # Обработанные датасеты
│   └── models/              # Сохранённые веса модели (.h5)
├── tests/
│   ├── test_auth.py         # Тесты авторизации
│   ├── test_model.py        # Тесты предсказаний
│   └── test_routes.py       # Тесты API-маршрутов
├── config.py                # Конфигурация приложения
├── requirements.txt         # Зависимости Python
├── run.py                   # Точка входа для запуска
├── .gitignore               # Исключаемые файлы
└── README.md                # Этот файл
```

---

## 🚀 Установка и запуск

### 1. Клонирование репозитория

```bash
git clone https://github.com/your-team/alien-classifier.git
cd alien-classifier
```

### 2. Создание виртуального окружения

```bash
python -m venv venv
source venv/bin/activate  # Linux/macOS
# или
venv\Scripts\activate     # Windows
```

### 3. Установка зависимостей

```bash
pip install -r requirements.txt
```

### 4. Настройка конфигурации

Создайте файл `.env` на основе `.env.example`:

```bash
cp .env.example .env
```

Заполните переменные:
```env
FLASK_APP=run.py
FLASK_ENV=development
SECRET_KEY=your-secret-key-here
DATABASE_URL=sqlite:///data/db.sqlite3
YDS_ENDPOINT=https://datasphere.api.cloud.yandex.net
YDS_ACCESS_KEY=your-access-key
YDS_SECRET_KEY=your-secret-key
```

### 5. Инициализация базы данных

```bash
flask db upgrade
# или вручную:
python -c "from app import db; db.create_all()"
```

### 6. Запуск приложения

```bash
python run.py
# или
flask run --host=0.0.0.0 --port=5000
```

🌐 Приложение доступно по адресу: `http://localhost:5000`

---

## 🎮 Использование

### 🔐 Авторизация

1. Перейдите на `/login`
2. Введите учетные данные:
   - **Администратор (по умолчанию)**:  
     `admin / admin123` *(смените пароль после первого входа!)*
   - **Пользователь**: создаётся администратором через панель `/admin/users`

### 👨‍💼 Панель администратора

- Перейдите в `/admin`
- Заполните форму: `Имя`, `Фамилия`, `Логин`, `Пароль`
- Новый пользователь появится в БД и сможет авторизоваться

### 👤 Панель пользователя

1. **Загрузка тестовых данных**
   - Перейдите в `/user/predict`
   - Загрузите файл `.npz` с массивом `test_x`
   - Нажмите "Классифицировать"

2. **Просмотр аналитики**
   - Перейдите в `/user/analytics`
   - Доступны все 4 типа диаграмм с возможностью масштабирования

3. **Результаты**
   - Точность (`accuracy`) и потери (`loss`) на тестовом наборе
   - Таблица предсказаний: `[индекс] → предсказанный класс → уверенность]`

---

## 🌐 API

### Авторизация

| Метод | Эндпоинт | Описание | Тело запроса |
|-------|----------|----------|--------------|
| `POST` | `/api/login` | Вход пользователя | `{"username": "...", "password": "..."}` |
| `POST` | `/api/logout` | Выход из системы | — |

### Пользователь

| Метод | Эндпоинт | Описание | Ответ |
|-------|----------|----------|--------|
| `GET` | `/api/user/me` | Информация о текущем пользователе | `{"id": 1, "name": "...", "role": "user"}` |
| `POST` | `/api/predict` | Классификация загруженного файла | `{"accuracy": 0.94, "predictions": [...]}` |
| `GET` | `/api/analytics` | Получение данных для графиков | `{"accuracy_plot": [...], "class_distribution": {...}}` |

### Администратор

| Метод | Эндпоинт | Описание | Тело запроса |
|-------|----------|----------|--------------|
| `POST` | `/api/admin/users` | Создание нового пользователя | `{"first_name": "...", "last_name": "...", "username": "...", "password": "..."}` |

> 🔐 Все эндпоинты, кроме `/api/login`, требуют заголовок `Authorization: Bearer <token>`

---

## 🧪 Тестирование

### Запуск unit-тестов

```bash
# Все тесты
pytest tests/

# С выводом покрытия
pytest --cov=app tests/

# Один файл тестов
pytest tests/test_model.py -v
```

### Пример теста модели

```python
# tests/test_model.py
def test_signal_prediction():
    model = load_model('data/models/alien_net.h5')
    sample = np.load('data/processed/sample_signal.npy')
    prediction = model.predict(sample.reshape(1, *sample.shape))
    assert prediction.shape == (1, NUM_CLASSES)
    assert np.all((prediction >= 0) & (prediction <= 1))
```

---

## ☁️ Развёртывание в Yandex DataSphere

### 1. Подготовка окружения

```bash
# Установите yc-cli и авторизуйтесь
yc init

# Создайте сервисный аккаунт с ролью editor
yc iam service-account create --name datasphere-runner
yc iam service-account add-role --role editor --service-account-name datasphere-runner
```

### 2. Загрузка данных

```python
# utils/data_uploader.py
import yandexcloud
from yandex.cloud.storage.v1.bucket_service_pb2 import ListBucketsRequest

sdk = yandexcloud.SDK()
# ... загрузка .npz-файлов в Object Storage
```

### 3. Обучение модели

```python
# scripts/train_in_datasphere.py
from tensorflow import keras

# Загрузка данных из облака
train_x, train_y = load_from_s3('s3://your-bucket/train.npz')

# Построение модели (без готовых архитектур!)
model = keras.Sequential([
    keras.layers.Input(shape=(SIGNAL_LENGTH,)),
    keras.layers.Conv1D(32, 3, activation='relu'),
    keras.layers.GlobalAveragePooling1D(),
    keras.layers.Dense(64, activation='relu'),
    keras.layers.Dense(NUM_CLASSES, activation='softmax')
])

model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
history = model.fit(train_x, train_y, epochs=50, validation_split=0.2)

# Сохранение
model.save('alien_net.h5')
```

### 4. Экспорт модели и артефактов

```bash
# После обучения в DataSphere:
yc storage object put --key models/alien_net.h5 --source alien_net.h5 --bucket your-bucket
```

---

## 📦 Сборка и деплой

### Создание Docker-образа (опционально)

```dockerfile
# Dockerfile
FROM python:3.10-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
RUN python -c "from app import db; db.create_all()"

EXPOSE 5000
CMD ["python", "run.py"]
```

```bash
docker build -t alien-classifier .
docker run -p 5000:5000 --env-file .env alien-classifier
```

---

## 🤝 Вклад в проект

1. Создайте ветку для фичи: `git checkout -b feature/amazing-feature`
2. Внесите изменения и добавьте тесты
3. Запустите тесты: `pytest`
4. Закоммитьте: `git commit -m 'Add: amazing feature'`
5. Отправьте: `git push origin feature/amazing-feature`
6. Создайте Pull Request

> ✅ Перед коммитом убедитесь, что:
> - Все тесты проходят
> - Код отформатирован (`black .`)
> - Нет чувствительных данных в коммитах

---

## 📄 Лицензия

Проект разработан в образовательных целях в рамках олимпиады МПОШ.  
Использование кода разрешено только участникам и жюри олимпиады.

> ⚠️ **Важно**: Обучающие данные и тестовые наборы защищены паролем и выдаются экспертной комиссией. Не распространяйте их.

---

## 🆘 Поддержка и контакты

- 📧 Вопросы по заданию: `support@olimp.miet.ru`
- 💬 Чат участников: [ссылка в личном кабинете]
- 🌐 Документация: [olimp.miet.ru/ppo_it](https://olimp.miet.ru/ppo_it)
```
