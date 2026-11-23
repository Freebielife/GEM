# Gem (GEM) Observatory

Независимая обсерватория токена GEM в сети TON. Основа: [TON-Observatory-Template](https://github.com/Freebielife/TON-Observatory-Template), версия **1.3.0**.

## О проекте

GEM — токен проекта Gem в сети TON. В исторических публикациях Gem • Global команда описывала Gem Chain как EVM L2 для TON и анонсировала DEX и использование GEM в ликвидности. Это заявления проекта, а не подтверждение текущей работы этих продуктов. На дату проверки сайт gem.bot представляет AI-ассистента в Telegram; актуальная роль GEM на сайте не установлена. Название Gem, символ GEM и точность 9 знаков сверены по метаданным указанного контракта.

Проверено: **2026-11-23**. Источники:

- https://tonapi.io/v2/jettons/EQB8O0JJ-hqeDAqDC1OG6zPYBfpV-QzwPed0kpcbILXsmAxG
- https://t.me/s/GemHQ
- https://tonscan.org/jetton/EQB8O0JJ-hqeDAqDC1OG6zPYBfpV-QzwPed0kpcbILXsmAxG
- https://gem.bot/

## Идентификация

- Контракт: `EQB8O0JJ-hqeDAqDC1OG6zPYBfpV-QzwPed0kpcbILXsmAxG`.
- Raw: `0:7c3b4249fa1a9e0c0a830b5386eb33d805fa55f90cf03de77492971b20b5ec98`.
- Метаданные: Gem / GEM, decimals 9.
- Канал владельцем указан как https://t.me/GemOfTonRu — используется в первом блоке и полезных ссылках.
- Главная карточка и эмблемы разделов: присланный пользователем `image(8).png`, явно одобренный для всех блоков. Оригинальный URL из метаданных сохранён как справочный; изображение оттуда не скачано, поскольку загрузка заблокирована в среде сборки.

## Данные и интерфейс

Операции buy/sell собираются для подтверждённых прямых GEM/TON пулов STON.fi и DeDust. Первичный пул для графика: `EQATwtlGQ05fjO7CRsn8FLc_fZ1MI-wahnLU_fk3ZFXgi3ua` (STON.fi), выбран по индексируемой USD-ликвидности среди подтверждённых TON-пар. Подтверждение обменов и источники сохранены в project.json. Другие пары могут присутствовать в списке пулов, но их обмены не заявляются как покрытые лентой.

RU/EN, самостоятельный index.html, покупки/продажи/сжигания, график оценки капитализации, холдеры 10→20, общие метки OG / Fragment +888 / четырёхзначные .ton / сжигания. Известные сервисы классифицируются сначала по Tonkeeper accounts.json; источник сохраняется. Оценка капитализации — цена последнего обмена первичного пула × текущая общая эмиссия, а не circulating market cap. История накапливается; неполное покрытие явно показывается. Сбои источников не заменяют исправные разделы пустыми данными.

## Сборка

```sh
python3 -m scripts.refresh_observatory
python3 build.py
python3 verify.py
python3 -m unittest discover -s tests -p 'test_*.py'
node --test tests/*.test.cjs
```

Ресурсы отображения встроены в HTML. Для обновления снимка и ручного поиска кошелька нужны сетевые запросы. SHA-256 и размер HTML проверяются в build/report.json при сборке.

## Публикация и обновления

GitHub Actions: `.github/workflows/update.yml`, запуск по изменению исходников и вручную. Он собирает данные, проверяет HTML и публикует data/snapshot.json и index.html в этот репозиторий. Публичный снимок: https://raw.githubusercontent.com/Freebielife/GEM/main/data/snapshot.json.

`scheduler-registration.json` — подготовленная запись для существующего Cloudflare-планировщика (30 минут). Её наличие **не подтверждает подключение**: нужен доступ к действующему Worker, сохранение полного его реестра и проверка реального запуска. Эта сборка не создаёт новый Worker и не меняет другие обсерватории.

TON Storage / Resistance Tools: публикация bag и привязка домена отдельно; сохранение кода в GitHub само по себе не публикует TON Site.
