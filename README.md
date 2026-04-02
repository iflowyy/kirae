# sori — visual author

Сайт-портфолио на Vue 3 + Vite.

## Запуск

```bash
npm install
npm run dev
```

Открой в браузере: http://localhost:5173

## Структура

```
sori/
├── src/
│   ├── App.vue
│   ├── main.js
│   ├── assets/main.css
│   └── components/
│       ├── NavBar.vue
│       ├── HeroSection.vue
│       ├── RainbowSection.vue
│       ├── CarouselSection.vue
│       ├── FeaturesSection.vue
│       ├── FaqSection.vue
│       └── FooterSection.vue
├── public/
│   └── videos/        ← сюда кладёшь свои mp4
├── task/
│   ├── task.md
│   └── terms.md
├── index.html
├── vite.config.js
└── package.json
```

## Как добавить своё видео в карусель

1. Положи mp4-файл в папку `public/videos/`, например `public/videos/silence.mp4`
2. Открой `src/components/CarouselSection.vue`
3. Найди массив `slides` и укажи путь:
   ```js
   { tag: 'Монтаж · 2025', caption: 'Silence — Атмосфера. Ритм.', grad: 'g1', video: '/videos/silence.mp4' },
   ```
4. Сохрани — видео появится в слайде вместо заглушки

**Рекомендуемые параметры видео:**
- Разрешение: 1280×720 или 1920×1080
- Формат: mp4, кодек H.264
- Продолжительность: 10–30 сек (зациклено)
- Размер: до 15 МБ на ролик
