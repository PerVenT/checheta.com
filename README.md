# checheta.com

Сайт Тані Чечети на Hugo. Шаблони, стилі й скрипти — у темі [hugo-checheta-theme](https://github.com/PerVenT/hugo-checheta-theme) (Hugo Module); тут лише контент і налаштування.


## Перевірка перед комітом

Хук `.githooks/pre-commit` збирає сайт; якщо поле задовге, закріплено два продукти чи посилання на відео не розпізнано — коміт не пройде, а в терміналі буде написано, що виправити. Увімкнути один раз на клон:

```sh
git config core.hooksPath .githooks
git add --chmod=+x .githooks/pre-commit
```

Та сама перевірка працює в `hugo server` одразу після збереження файлу.

## Де що лежить

| Сторінка | Файл |
| --- | --- |
| Головна | `content/_index.md` (`hero`) |
| Шапка профілю `/links` | `content/links.md` |
| Продукти | `content/products/*.md` |
| Безкоштовні уроки | `content/lessons/*.md` |
| Про мене | `content/about.md` |
| Контакти | `content/contacts.md` + `params.email`, `params.telegram` у `hugo.yml` |
| «Дякую» після оплати / реєстрації | `content/thanks/payment.md`, `registration.md` |
| Оферта, конфіденційність, повернення | `content/offer.md`, `privacy.md`, `refund.md` |
| Меню шапки й футера | `menus` у `hugo.yml` |
| Фото продуктів | `assets/images/products/<id>.jpg` і `<id>-dark.jpg` — підхоплюються самі |
| Інші фото | `assets/images/` (шлях у полях — `images/назва.jpg`) |

## Як редагувати продукт

Усе, що бачить відвідувачка на картці й угорі сторінки, — у полях на початку файлу (front matter). Текст після другого `---` — довгий опис під шапкою сторінки.

Новий продукт — копія шаблону свого типу: `content/products/template_mentorship.md`, `template_mini.md`, `template_game.md`, `template_webinar.md`, урок — `content/lessons/template_lesson.md`. 

> [!warning] У шаблонах прокоментовані всі поля
> Блок `build` у копії прибери, інакше сторінка не з'явиться на сайті.

| Поле | Що це |
| --- | --- |
| `title` | Назва (до 55 символів) |
| `id` | Стабільний ідентифікатор для аналітики й n8n — не змінювати |
| `product_type` | `mentorship`, `mini`, `game`, `webinar` |
| `status` | `open` — продаж/реєстрація, `waitlist` — «Скоро новий набір» з формою, `close` — прихований зі списків |
| `start` | Дата старту, напр. `2026-11-25` або `2026-11-15T11:00:00+02:00`; набір закривається зі стартом, за 7 днів з'являється відлік |
| `pinned: true` | Показувати першим і після старту (лише один продукт на сайт); позначається вдавленим лотосом |
| `price` | Ціна в грн — на кнопці «Оплатити · 999 грн» |
| `payment.url` | Посилання на кнопку WayForPay (`https://secure.wayforpay.com/button/…`, без HTML-коду); `mode: widget` — оплата у вікні поверх сайту, `link` — перехід на сторінку оплати; повернення після оплати — `https://checheta.com/thanks/payment/` |
| `lead` | Короткий опис під заголовком (до 160 символів), він же опис для Google |
| картинка | Файл `assets/images/products/<id>.jpg` (jpg, png або webp), для темної теми — `<id>-dark.jpg`. Поле `image` / `image_dark` потрібне, лише якщо хочеш інший файл |
| `bonus`, `chips` | Рядок із подарунком і до 3 міток |
| `program`, `audience`, `results`, `faq`, `testimonials` | Розділи сторінки |

Ліміти довжини всіх полів — у README теми. Текст зі списку, у якому є кома, пишіть стовпчиком через `- `, а не в `[…]`.

Порядок на головній: закріплений → ті, що ще не стартували (за датою) → без дати (за `weight`). Відкритий вебінар сам показує форму реєстрації.
