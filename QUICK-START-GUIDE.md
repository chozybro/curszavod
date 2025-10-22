# ⚡ Быстрый старт - SEO Контент-Завод

## 5 минут до первой статьи!

### Шаг 1: Подготовка API ключей (2 минуты)

#### OpenAI API Key
1. Перейдите: https://platform.openai.com/api-keys
2. Нажмите "Create new secret key"
3. Скопируйте ключ (сохраните в безопасное место!)
4. Пополните баланс минимум на $5: https://platform.openai.com/account/billing

#### WordPress Application Password
1. Войдите в WordPress Admin
2. Users → Your Profile
3. Прокрутите до "Application Passwords"
4. Введите имя: "n8n automation"
5. Нажмите "Add New Application Password"
6. Скопируйте сгенерированный пароль

### Шаг 2: Создание Google Sheets (1 минута)

1. Откройте: https://sheets.google.com
2. Создайте новую таблицу
3. Скопируйте содержимое из файла `google-sheets-template.csv`
4. Вставьте в первую строку таблицы
5. Скопируйте ID таблицы из URL:
   ```
   https://docs.google.com/spreadsheets/d/[ВОТ_ЭТОТ_ID]/edit
   ```

### Шаг 3: Импорт в n8n (2 минуты)

1. Откройте n8n
2. Workflows → Import from File
3. Выберите `seo-content-factory-n8n.json`
4. Workflow импортирован! ✅

### Шаг 4: Быстрая настройка (2 минуты)

#### 4.1 OpenAI Credential
1. Откройте любую ноду с OpenAI (например, "AI Research Topic")
2. В поле "Credential to connect with" → "Create New"
3. Вставьте ваш API Key
4. Нажмите "Save"
5. Выберите этот credential во ВСЕХ OpenAI нодах

#### 4.2 Google Sheets Credential
1. Откройте ноду "Read Topics from Google Sheets"
2. "Credential to connect with" → "Create New"
3. Следуйте OAuth процессу (разрешите доступ)
4. Выберите этот credential во всех Google Sheets нодах

#### 4.3 WordPress Credential
1. Откройте ноду "Publish to WordPress"
2. "Credential to connect with" → "Create New"
3. Заполните:
   - **Username**: ваш WordPress username
   - **Password**: Application Password из Шага 1
   - **URL**: https://your-site.com (БЕЗ /wp-admin!)
4. Нажмите "Save"
5. Выберите этот credential во всех WordPress нодах

#### 4.4 Вставка ID Google Sheets
1. Используйте функцию "Find and Replace" в n8n (Ctrl+F)
2. Найдите: `YOUR_GOOGLE_SHEET_ID`
3. Замените на: ваш ID из Шага 2
4. Replace All

#### 4.5 Вставка WordPress URL
1. Find and Replace (Ctrl+F)
2. Найдите: `https://YOUR-WORDPRESS-SITE.com`
3. Замените на: `https://your-actual-site.com`
4. Replace All

### Шаг 5: Тест! (1 минута)

1. Нажмите "Execute Workflow" в правом верхнем углу
2. Наблюдайте как магия происходит! 🎉
3. Через 2-3 минуты статья будет опубликована

### Проверка результата:

1. Откройте вашу Google таблицу
2. Статус должен измениться на "Published"
3. В колонке "ArticleURL" появится ссылка
4. Перейдите по ссылке → ваша статья опубликована! 🚀

---

## 🎯 Что дальше?

### Автоматизация
1. В ноде "Schedule Trigger" активируйте расписание
2. Добавьте больше тем в Google Sheets
3. Workflow будет работать автоматически!

### Оптимизация
1. Прочитайте `README-SEO-ZAVVOD.md` для детальных настроек
2. Настройте качество AI под ваши нужды
3. Экспериментируйте с промптами!

---

## ❓ Частые ошибки

**Ошибка: "Invalid API Key"**
→ Проверьте баланс OpenAI и правильность ключа

**Ошибка: "Authentication failed" (WordPress)**
→ Убедитесь что URL без /wp-admin и Application Password скопирован полностью

**Ошибка: "Sheet not found"**
→ Проверьте что ID таблицы скопирован правильно

**Статья публикуется без изображений**
→ Проверьте что в WordPress разрешена загрузка файлов

---

## 💡 Совет Pro:

Первые 2-3 статьи публикуйте в черновики (`status: "draft"`), чтобы проверить качество и отрегулировать промпты!

**Готово! Теперь у вас есть полноценный SEO контент-завод! 🎊**
