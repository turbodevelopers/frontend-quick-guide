## Типовая структура проекта

Прежде, чем говорить о верстке, необходимо описать типовую структуру проекта.

```
templates                           # Весь фронтенд проекта
    ├── build/                      # Итоговые файлы для разработки и продакшена. Здесь не нужно ничего трогать, т.к. все файлы пересобираются сборщиком автоматически.
        ├── css/                    # Итоговые css файлы (dev и min версии)
        ├── js/                     # Итоговые js файлы (dev и min версии)
        └── images/                 # Сжатые картинки и итоговые спрайты (копируются из папки templates/images/)
    ├── components/                 # PHP компоненты проекта
    ├── fonts/                      # Шрифты, если шрифтов несколько, то лучше разложить их по папкам
    ├── gulp/                       # Вспомогательные Gulp таски, сюда лезть скорее всего не придется, т.к. из коробки все что нужно уже настроено
        ├── core/                   # Обертка для Gulp, добавляющая некоторые возможности и упрощающая разработку
        ├── modules/                # Таски для PNG и SVG спрайтов
        └── utils/                  # Gulp утилиты
    ├── images/                     # Картинки для dev сборки, лучше раскладывать их по папкам
        ├── png-sprites/            # PNG спрайты
        ├── sprite.svg              # SVG спрайт для подключения в LESS
        └── symbols.svg             # SVG спрайт для подключения в HTML
    ├── pages/                      # PHP страницы проекта
    ├── sprites/                    # Исходники для спрайтов
        ├── png/                    # Картинки для PNG спрайтов
        └── svg/                    # Картинки для SVG спрайтов
    ├── src/                        # Исходный код проекта
        ├── js/                     # Скрипты
            ├── BView/              # Backbone Views ("вьюхи")
                └── subView/        # "Сабвьюхи" - модули, которые могут использоваться в нескольких вьюхах
            ├── components/         # Компоненты
            ├── core/               # Базовые скрипты
            ├── libs/               # Сторонние библиотеки
            └── script.js           # Точка входа для скриптов (инициализация приложения)
        ├── less/                   # Стили
            ├── core/               # Базовые стили (normalize, шрифты, спрайты и т.п.)
            ├── common/             # Базовые модули (header, footer и т.п.)
            ├── modules/            # Все остальные модули
            ├── libs/               # Стили библиотек и плагинов
            └── styles.less         # Точка входа для стилей        
    ├── BODY.tpl.php                # Точка входа для PHP страниц
    └── gulpfile.js                 # Основные Gulp таски для сборки проекта
```


