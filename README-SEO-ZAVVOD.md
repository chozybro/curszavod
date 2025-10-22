# 🚀 SEO Контент-Завод через n8n

Автоматизированная система для создания и публикации SEO-оптимизированного контента с использованием AI.

## 📋 Что делает этот workflow?

1. **Читает темы из Google Sheets** - автоматически берет темы для статей
2. **AI исследование темы** - изучает тему, собирает статистику и факты
3. **Генерация статьи** - создает полноценную SEO-оптимизированную статью
4. **Создание изображений** - генерирует 4 уникальных изображения для статьи
5. **Публикация в WordPress** - автоматически публикует на ваш сайт
6. **Обновление статуса** - отмечает выполненные задачи в Google Sheets

---

## 🛠️ Требования

### 1. **API Ключи**
- ✅ OpenAI API Key (для GPT-4 и DALL-E)
  - Получить: https://platform.openai.com/api-keys
  - Необходим платный аккаунт с балансом
  
### 2. **Google Sheets**
- ✅ Google Cloud проект с включенным Google Sheets API
- ✅ OAuth2 credentials для n8n

### 3. **WordPress**
- ✅ Self-hosted WordPress сайт
- ✅ Application Password для API доступа
  - Как создать: WordPress Admin → Users → Profile → Application Passwords

### 4. **n8n**
- ✅ Установленный n8n (версия 1.0+)
- ✅ Необходимые ноды установлены (обычно идут из коробки)

---

## 📊 Структура Google Sheets

Создайте Google таблицу со следующими колонками:

| Topic | Keywords | Title | Language | WordCount | Status | ArticleURL | PublishDate | ErrorMessage |
|-------|----------|-------|----------|-----------|--------|------------|-------------|--------------|
| Как выбрать CRM систему | crm, система, бизнес | Полное руководство по выбору CRM | Russian | 2500 | Pending | | | |
| Best SEO tools 2024 | seo, tools, marketing | Top 10 SEO Tools for 2024 | English | 3000 | Pending | | | |

### Описание колонок:

- **Topic** (обязательно) - Основная тема статьи
- **Keywords** (обязательно) - Ключевые слова через запятую
- **Title** (обязательно) - Заголовок статьи
- **Language** (опционально) - Язык статьи (по умолчанию: Russian)
- **WordCount** (опционально) - Количество слов (по умолчанию: 2000)
- **Status** - Статус (Pending/Published/Error)
- **ArticleURL** - URL опубликованной статьи (заполняется автоматически)
- **PublishDate** - Дата публикации (заполняется автоматически)
- **ErrorMessage** - Сообщение об ошибке (если есть)

---

## ⚙️ Настройка Workflow

### Шаг 1: Импорт в n8n

1. Откройте n8n
2. Нажмите на меню (три точки) → Import from File
3. Выберите файл `seo-content-factory-n8n.json`

### Шаг 2: Настройка Credentials

#### 2.1 OpenAI API
1. Откройте любую ноду с OpenAI
2. Кликните на "Create New Credential"
3. Введите ваш OpenAI API Key
4. Сохраните

#### 2.2 Google Sheets OAuth2
1. Откройте ноду "Read Topics from Google Sheets"
2. Кликните на "Create New Credential"
3. Следуйте инструкциям n8n для OAuth2 авторизации
4. Авторизуйтесь через Google аккаунт

#### 2.3 WordPress API
1. В WordPress: User → Profile → Application Passwords
2. Создайте новый пароль (например, "n8n automation")
3. Скопируйте сгенерированный пароль
4. В n8n откройте ноду "Publish to WordPress"
5. Создайте credential:
   - Username: ваш WordPress username
   - Password: скопированный Application Password
   - URL: https://your-site.com

### Шаг 3: Настройка нод

Замените следующие значения во всех нодах:

#### Google Sheets ноды:
- `YOUR_GOOGLE_SHEET_ID` → ID вашей таблицы (из URL)
- `YOUR_GOOGLE_SHEETS_CREDENTIAL_ID` → выберите созданный credential

#### OpenAI ноды:
- `YOUR_OPENAI_CREDENTIAL_ID` → выберите созданный credential

#### WordPress ноды:
- `https://YOUR-WORDPRESS-SITE.com` → URL вашего сайта
- `YOUR_WORDPRESS_CREDENTIAL_ID` → выберите созданный credential

### Шаг 4: Настройка расписания

В ноде "Schedule Trigger":
- По умолчанию: каждые 6 часов
- Можете изменить на любой интервал

---

## 🎯 Как использовать

### Автоматический режим:
1. Добавьте темы в Google Sheets со статусом "Pending"
2. Workflow автоматически будет обрабатывать по 1 теме каждые 6 часов
3. После публикации статус изменится на "Published"
4. URL статьи будет добавлен в таблицу

### Ручной запуск:
1. Откройте workflow в n8n
2. Нажмите "Execute Workflow"
3. Workflow обработает одну тему со статусом "Pending"

---

## 💰 Примерная стоимость

### За одну статью (2000 слов + 4 изображения):

**OpenAI GPT-4o:**
- Research (2000 tokens): ~$0.01
- Article generation (4000 tokens): ~$0.02
- Image prompts (500 tokens): ~$0.005
- **Итого текст: ~$0.035**

**DALL-E 3:**
- 4 изображения 1024x1024: 4 × $0.04 = $0.16
- **Итого изображения: $0.16**

**Общая стоимость: ~$0.20 за статью**

### Месячные затраты:
- 10 статей/месяц: ~$2
- 50 статей/месяц: ~$10
- 100 статей/месяц: ~$20

---

## 🔧 Кастомизация

### Изменить AI модель:
В нодах AI можно изменить модель:
- `gpt-4o` - самая мощная, дорогая
- `gpt-4o-mini` - быстрая и дешевая
- `gpt-3.5-turbo` - самая дешевая

### Изменить качество изображений:
В ноде "Generate Images (DALL-E)":
- `quality: "hd"` - высокое качество (дороже)
- `quality: "standard"` - стандартное (дешевле)

### Изменить количество изображений:
В ноде "Generate Image Prompts" измените число в промпте:
```
Generate 4 detailed image prompts
```
на нужное вам (от 1 до 10).

### Публикация в черновики вместо автопубликации:
В ноде "Publish to WordPress" измените:
```json
"status": "draft"  // вместо "publish"
```

---

## 🐛 Troubleshooting

### Проблема: "Invalid API Key"
**Решение:** Проверьте правильность API ключа OpenAI и наличие баланса

### Проблема: "Rate limit exceeded"
**Решение:** Увеличьте интервал между запусками workflow

### Проблема: "WordPress authentication failed"
**Решение:** 
- Проверьте Application Password
- Убедитесь что REST API включен в WordPress
- Проверьте URL (должен быть без trailing slash)

### Проблема: Статья не публикуется
**Решение:** 
- Проверьте логи n8n
- Убедитесь что пользователь WordPress имеет права на публикацию
- Проверьте что контент валиден (нет запрещенных HTML тегов)

### Проблема: Изображения не загружаются
**Решение:**
- Проверьте что WordPress разрешает загрузку файлов
- Увеличьте upload_max_filesize в PHP
- Проверьте права на папку wp-content/uploads

---

## 🎨 Альтернативные сервисы

### Вместо OpenAI GPT:
- **Claude (Anthropic)** - используйте ноду `@n8n/n8n-nodes-langchain.lmChatAnthropic`
- **Google Gemini** - используйте ноду `@n8n/n8n-nodes-langchain.lmChatGoogleGemini`
- **Local LLM** - используйте Ollama ноду для локальных моделей

### Вместо DALL-E:
- **Stable Diffusion** - используйте HTTP Request к Stability AI API
- **Leonardo.ai** - используйте HTTP Request к Leonardo API
- **Midjourney** - требует Discord интеграцию (сложнее)

---

## 📝 Примеры промптов для улучшения качества

### Для исследования темы:
```
You are an expert SEO researcher with 10+ years of experience. 
Research this topic like you're writing for Forbes or TechCrunch.
Include only verified facts and recent statistics (2023-2024).
```

### Для написания статьи:
```
You are an award-winning content writer and SEO expert.
Write in a conversational yet professional tone.
Use storytelling techniques to engage readers.
Include real-world examples and case studies.
```

---

## 🔐 Безопасность

1. **Не коммитьте credentials в Git**
2. **Используйте переменные окружения** для чувствительных данных
3. **Регулярно меняйте API ключи**
4. **Ограничьте права WordPress пользователя** только необходимыми
5. **Включите Rate Limiting** в n8n для защиты от перерасхода

---

## 📈 Масштабирование

### Для обработки большого объема:

1. **Параллельная обработка**: 
   - Измените "Limit to 1 Topic" на больше тем
   - Добавьте Split in Batches ноду

2. **Очередь задач**:
   - Используйте Redis Queue
   - Настройте webhook триггер

3. **Множественные WordPress сайты**:
   - Добавьте колонку "TargetSite" в Google Sheets
   - Используйте Switch ноду для роутинга

---

## 🆘 Поддержка

Если возникли вопросы:
1. Проверьте логи в n8n
2. Убедитесь что все credentials настроены
3. Протестируйте каждую ноду отдельно
4. Проверьте баланс OpenAI

---

## 📜 Лицензия

MIT License - используйте свободно для коммерческих и личных проектов.

---

**Создано с ❤️ для автоматизации контент-маркетинга**

*Версия: 1.0.0 | Дата: 2025-10-22*
