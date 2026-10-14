# ДЗ7 — Звірковська Ірина

## Дані
Реальний NYC TLC Yellow Taxi Parquet за березень 2024 року:
https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

Файл завантажується кодом з офіційного CDN. Після обмеження дат березнем відбираються 500 000 випадкових поїздок (`random_state=42`), потім застосовується очищення fare/distance. Залишилося 480 094 поїздки. Stub fallback не використано. Parquet до архіву не включено.

## Зміст
- Daily aggregation і повний календар: 248 зон × 31 день = 7 688 рядків.
- Lag 1/7/30, rolling average 7 днів, volatility 30 днів, expanding sum/average та combined view.
- 50 000 синтетичних JSONB-подій, 5 типів, containment, key existence і JSONPath.
- GIN та expression B-tree: повні EXPLAIN (ANALYZE, BUFFERS) до і після індексації.
- Normalized checkout, перевірка однакових результатів і обидва EXPLAIN.
- Reflection 250–300 слів за фактичними результатами.

## Запуск
1. Завантажити notebook у Google Colab.
2. Обрати Runtime → Restart session and run all.
3. Дочекатися завершення всіх комірок і зберегти notebook з outputs.

Перша комірка встановлює залежності та запускає pgserver. Дані зберігаються в /content у Colab або в hw7_data поруч із notebook локально. Існуючий Parquet використовується повторно. Навчальні таблиці, view та індекси перевідтворюються автоматично. Потрібен інтернет для встановлення пакетів і першого завантаження даних.

## Перевірка
Notebook двічі успішно виконано з новим ядром локально: macOS, Python 3.12.14, PostgreSQL 16.2. Усі 23 кодові комірки виконані, помилок немає, 7 повних EXPLAIN збережено. Перевірені календарні lag-ознаки та рівність JSONB/normalized результатів. Google Colab Restart & Run All не перевірено. Reflection описує збережений локальний запуск; нові вимірювання можуть відрізнятися.

Публічний репозиторій і завантаження в LMS не виконувалися.
