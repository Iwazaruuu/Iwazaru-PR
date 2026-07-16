# Iwazaru Portfolio

Одностраничный сайт-портфолио на Vue 3 + Vite + GSAP.

## Деплой

Сайт задеплоен на GitHub Pages: https://iwazaruuu.github.io/Iwazaru-PR/

## Как обновить картинки

### 1. Добавить или удалить файлы

Картинки лежат в папке `public/portfolio/images/`. Ты можешь:

- **Добавить** — перетащить новые `.png` или `.jpg` в эту папку (или в подпапку, например `public/portfolio/images/НовыйПроект/`)
- **Удалить** — просто удалить файл из папки

**Важно:** используй только латиницу в именах файлов и папок. Пробелы можно.

### 2. Обновить код

Открой `src/components/ProjectsSection.vue`. Внутри массив `projects` — каждый проект выглядит так:

```js
{
  id: 'fixlab',
  title: 'FixLab',
  desc: 'Описание...',
  dir: import.meta.env.BASE_URL + 'portfolio/images/FixLab',
  images: [
    'fixlab_ru_final.png',
    'fixlab_LV_final.png',
  ]
}
```

**Удалить картинку** — убери строчку из массива `images`.

**Добавить картинку** — допиши имя файла в `images`.

**Добавить новый проект** — скопируй блок и замени `id`, `title`, `desc`, `dir`, `images`.

### 3. Задеплоить

Открой терминал в папке проекта и выполни:

```bash
npm run build
git add .
git commit -m "обновил картинки"
git push
```

Через 30-60 секунд изменения появятся на сайте.

## Разработка локально

```bash
npm install
npm run dev
```

Откроется на http://localhost:5173