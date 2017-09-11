# Разворачивание проекта

1. Скачать репозиторий [libs](http://hg.turbodevelopers.com/turbo/libs)
1. Перейти в крайнюю ревизию ветки `configurable-build`
1. В корне локального веб-сервера Apache (`DOCUMENT_ROOT`) создать папку для нового проекта, скопировать туда все содержимое из `libs`.
1. Если все сделано правильно, то сайт с дефолтной версткой станет доступен по адресу `http://127.0.0.1/<папка_проекта>`
1. В терминале перейти в `<папка_проекта>/templates/` и запустить `npm install` (или просто `npm i`) для установки npm модулей.  

Обратите внимание, что при запуске `npm i` загрузятся абсолютно все модули, указанные в `templates/package.json`. Однако, есть и опциональные модули, скачивать которые не обязательно. Они описаны в объекте `optionalDependencies`.
```json
{
  "devDependencies": {
    "core": "file:gulp\\core"                                  # Базовые пакеты для разработки
  },
  "optionalDependencies": {                                    # Опциональные пакеты
    "gulp-less": "^3.3.0",                                     # LESS
    "gulp-sass": "^3.1.0",                                     # Sass
    "gulp-stylus": "^2.6.0",                                   # Stylus
    "done_message": "file:gulp\\modules\\done_message",        # 
    "jade-templates": "file:gulp\\modules\\jade-templates",    # Пакеты для сборки Jade
    "png-sprite": "file:gulp\\modules\\png-sprite",            # Пакеты для сборки PNG спрайтов
    "svg-sprite": "file:gulp\\modules\\svg-sprite"             # Пакеты для сборки SVG спрайтов
  }
}

```

Если вы не хотите скачивать все опциональные модули, то нужно запускать установку с указанием конкретных пакетов через пробел: `npm i <имя_пакета_1> <имя_пакета_2>`. Например, вы решили, что будете писать обычный HTML, использовать Stylus в качестве препроцессора и собирать только SVG спрайты. Тогда нужно запустить команду `npm i core gulp-stylus svg-sprite`.