# kirae — visual author

Сайт-портфолио визуального автора и монтажёра .

## Установка
```bash
npm i
```

## Запуск
```bash
npm run dev
```

Открой в браузере : http://localhost:5173

## Сборка для продакшена
```bash
npm run build
```

## Структура проекта
```
src/
├── App.vue
├── main.js
├── assets/
│   └── main.css
└── components/
    ├── NavBar.vue
    ├── HeroSection.vue
    ├── RainbowSection.vue
    ├── CarouselSection.vue
    ├── FeaturesSection.vue
    ├── FaqSection.vue
    └── FooterSection.vue
public/
└── videos/        ← сюда кладёшь свои mp4
```

## Как добавить видео

1. Положи файл в `public/videos/` , например `public/videos/project1.mp4`
2. Открой `src/components/CarouselSection.vue`
3. В массиве `slides` укажи путь : `video: '/videos/project1.mp4'`
