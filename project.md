# project.md — Паспорт проекта 2akva.ru

> Последнее обновление: март 2026

---

## 1. Что это за проект

Корпоративный сайт компании **ООО «2Н АКВА»** — производителя и поставщика оборудования для водоподготовки, насосных систем и дренажа (бренд **2H GEOdek**). Аудитория — B2B-клиенты: строительные компании, частные заказчики, монтажные организации.

---

## 2. Адреса и доступы

| Параметр | Значение |
|---|---|
| Сайт (продакшн) | https://2akva.ru |
| Локальный URL | http://2akva.local |
| Контактный e-mail | info@2akva.ru |
| Руководитель | Гагуа В.В. (Генеральный директор) |
| Владелец / разработчик | Andrey-don |

---

## 3. Техническая инфраструктура

### CMS и тема

| Параметр | Значение |
|---|---|
| CMS | WordPress 6.9.4 |
| Тема | 2akva (кастомная, без дочерней) |
| Папка темы | `wp-content/themes/2akva/` |
| Главная страница | ID: 42, post_name: glavnaja, шаблон: front-page.php |
| CPT | `equipment`, `areas_of_use` |

### Хостинг

| Параметр | Значение |
|---|---|
| Хостинг-провайдер | Sweb.ru (SpaceWeb) |
| Панель управления | cp.sweb.ru |
| IP-адрес | 77.222.62.59 |
| PHP | 8.3 |
| MySQL | 8.0 |
| SSL | Активен (HTTPS, redirect 301 через .htaccess) |

### DNS (управляются в cp.sweb.ru)

| Запись | Значение |
|---|---|
| NS | ns1.spaceweb.ru, ns2.spaceweb.ru, ns3.spaceweb.pro, ns4.spaceweb.pro |
| MX | mx.yandex.net (приоритет 10) — **НЕ менять!** |
| SPF | v=spf1 include:_spf.yandex.net include:spaceweb.ru ~all |
| DKIM | sweb._domainkey (TXT) |
| DMARC | v=DMARC1; p=none; rua=mailto:info@2akva.ru |
| Яндекс верификация | yamail-785f35779172.2akva.ru → mail.yandex.ru (CNAME) |

### Локальная среда

| Параметр | Значение |
|---|---|
| Среда | Local by Flywheel (Local WP) |
| Локальный URL | http://2akva.local |
| Путь | `C:/Users/profi/Local Sites/2akva/app/public/` |
| PHP (local) | 8.3.29 |
| MySQL (local) | 8.0.35 |

### Репозиторий

| Параметр | Значение |
|---|---|
| Git (локальный) | `C:/Users/profi/Documents/Project/2KVA` |
| Структура в репо | `site/public_html/` |
| GitHub | Andrey-don/my-akva |
| Ветка | master |

---

## 4. Плагины WordPress

> Плагины **не хранятся в Git** — устанавливать вручную при переносе.

| Плагин | Версия | Статус | Назначение |
|---|---|---|---|
| Advanced Custom Fields (ACF) | — | Активен | Кастомные поля |
| ACF Repeater | — | Активен | Повторяющиеся блоки на главной |
| Yoast SEO | 27.1.1 | Активен | SEO-оптимизация, XML-карта сайта |
| WP Mail SMTP | — | Активен | Отправка писем через Spaceweb SMTP |
| Contact Form 7 | — | Активен | Контактные формы (From/To: info@2akva.ru) |
| Really Simple Security | — | Активен | SSL, защита, mixed content fix |
| Duplicator | 1.5.15 | Неактивен (хранить!) | Резервное копирование и миграция |

---

## 5. Структура контента

### Страницы

| Страница | ID | Шаблон |
|---|---|---|
| Главная | 42 | front-page.php |
| Контакты | — | — |
| О компании | — | — |

### Custom Post Types

| CPT | Назначение |
|---|---|
| equipment | Каталог оборудования |
| areas_of_use | Области применения |

---

## 6. SEO и индексация

| Параметр | Значение |
|---|---|
| robots.txt | Настроен вручную |
| Карта сайта | https://2akva.ru/sitemap.xml (Yoast SEO) |
| Верификация Google | googlebd92a4a473fba094.html |
| Верификация Яндекс | yandex_4b1bfc2d42dec3a7.html (и ещё 2 файла) |

---

## 7. Что в Git, что нет

### Включено в репозиторий
- `wp-content/themes/2akva/` — кастомная тема
- `.htaccess`, `robots.txt`, `wp-config-sample.php`
- `googlebd92a4a473fba094.html`, `yandex_*.html` — файлы верификации

### Исключено (.gitignore)
- `wp-content/plugins/` — плагины (устанавливать вручную)
- `wp-content/uploads/` — медиафайлы (переносить вручную или через Duplicator)
- `wp-content/cache/`, `wp-content/upgrade/`, `wp-content/languages/`
- `wp-config.php` — содержит учётные данные БД, **не коммитить**
- `Буклеты/` — маркетинговые материалы

---

## 8. Важные предупреждения

- **MX-запись** — НЕ менять `mx.yandex.net`. Все сотрудники используют Яндекс 360 (@2akva.ru). Смена MX = потеря корпоративной почты.
- **wp-includes/class-wp-query.php** — содержит ручное исправление строка 756 (`intval()`). При обновлении WordPress — внести правку повторно.
- **jQuery** — в `functions.php` есть фильтр замены jQuery 4.0 → 3.7.1 (CDN). При обновлении темы — проверить наличие фильтра.
- **Медиафайлы** — не в Git. При переносе копировать `uploads/` вручную или через Duplicator.
- **Резервные копии** — перед обновлением WordPress или плагинов делать бэкап через Duplicator.

---

## 9. История коммитов

| Дата | Описание |
|---|---|
| Март 2026 | Fix PHP 8.2 compatibility for WordPress 5.3.x |
| Март 2026 | Fix nav menu walker, rewrite rules, and PHP 8.2 compatibility |
| Март 2026 | Update .gitignore to exclude Буклеты folder |
| Март 2026 | Add CPT registration for equipment and areas_of_use, fix hierarchical rewrite rules |
| Март 2026 | Fix news category page and excerpt_more button |
| Март 2026 | Fix Array link in areas_of_use archive page |
| Март 2026 | Hide GEOdek block on front page (no link = skip) |
| Март 2026 | Block public access to debug.log via .htaccess |
| Март 2026 | Fix jQuery 4.0 incompatibility with webflow.js |
| 17.03.2026 | Add project documentation: TZ, reports and project passport |
| 17.03.2026 | Add TZ and report documents for 2akva.ru technical support |

---

## Связанные файлы

- [CLAUDE.md](CLAUDE.md) — правила работы AI с проектом
- [ПАСПОРТ_ПРОЕКТА_2akva.ru.html](ПАСПОРТ_ПРОЕКТА_2akva.ru.html) — паспорт в HTML (для печати)
- [ТЗ_и_Отчет_2akva.ru.html](ТЗ_и_Отчет_2akva.ru.html) — ТЗ и отчёт о выполненных работах
