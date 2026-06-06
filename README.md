# TAKE — Bluetooth Camera App

Приложение для видеосъёмки с управлением через Bluetooth-пульт (или клавиатуру).

## Как работает

- **1 нажатие** → начало записи дубля
- **2 нажатие** → стоп, полупрозрачный оверлей
- **3 нажатие** → запись дубля 2 и т.д.
- **Кнопка «Удалить дубль»** → однократно удаляет последний дубль, двойной тап — удаляет 2 последних дубля
- **Кнопка «Монтаж»** → склеивает все дубли в одно видео и скачивает

## Поддержка Bluetooth-пультов

Поддерживаются пульты через:
- Клавиши: `Space`, `Enter`, `ArrowUp/Down`, `PageUp/Down`, `VolumeUp/Down`, медиа-клавиши
- Gamepad API (пульты, которые определяются как геймпад)

## Деплой на Cloudflare Workers через GitHub

### 1. Получить токены Cloudflare

1. Зайди на [dash.cloudflare.com](https://dash.cloudflare.com)
2. **Account ID** — на главной странице, правый сайдбар
3. **API Token** — My Profile → API Tokens → Create Token → шаблон «Edit Cloudflare Workers»

### 2. Добавить секреты в GitHub

В репозитории: Settings → Secrets and variables → Actions → New repository secret:

- `CLOUDFLARE_API_TOKEN` — твой API токен
- `CLOUDFLARE_ACCOUNT_ID` — твой Account ID

### 3. Загрузить в GitHub

```bash
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin https://github.com/ВАШ_ЮЗЕРНЕЙМ/bluetooth-cam.git
git push -u origin main
```

После пуша GitHub Actions автоматически задеплоит воркер на Cloudflare.

### 4. Имя воркера

В `wrangler.toml` поле `name = "bluetooth-cam"` — это субдомен воркера.
Приложение будет доступно по адресу:
```
https://bluetooth-cam.ВАШ_ПОДДОМЕН.workers.dev
```

## Локальный запуск

```bash
npm install
npm run dev
```

## Структура

```
├── src/
│   └── index.js          # Cloudflare Worker
├── public/
│   └── index.html        # Всё приложение
├── .github/
│   └── workflows/
│       └── deploy.yml    # Auto-deploy
├── wrangler.toml
└── package.json
```
