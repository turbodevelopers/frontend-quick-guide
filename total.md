## Итого

- Чтобы развернуть проект, нужно скачать репозиторий [libs](http://hg.turbodevelopers.com/turbo/libs), перейти в крайнюю ревизию ветки `altVersion-ks` и скопировать содержимое в папку нового проекта.
- Чтобы создать страницу новостей, нужно в `templates\pages` создать файл `news.php`. Страница станет доступна по адресу `имя_проекта/news`.
- Чтобы подключить стили к странице новостей, нужно в `templates\src\less\modules` создать файл `news.less`. Затем подключить этот файл в точке входа `templates\src\less\styles.less`.
- Чтобы подключить скрипты к странице новостей, нужно в `templates\src\js\BView` создать вьюху `News.js`. Затем на странице `news.php` добавить в корневой элемент `data-view="News"`.
- Чтобы подключить резину на ремах, нужно настроить объект `cfgs` в `templates\src\js\components\Adaptive.js`.
- Чтобы собрать PNG спрайт для страницы новостей, нужно в `templates\sprites\png\` создать папку `news` и положить в нее картинки. Чтобы подключить в LESS картинку `favorite.png`, нужно добавить миксин `.bg-png(@png-favorite)`.
- Чтобы собрать SVG спрайт, нужно в `templates\sprites\svg\` положить SVG картинки. Чтобы подключить в LESS картинку `favorite.svg`, нужно добавить миксин `.bg-svg(@svg-favorite)`. Чтобы подключить в HTML картинку `favorite.svg` нужно написать: `<svg><use xlink:href="http://<?=$_SERVER['HTTP_HOST'] . WWW_PATH?>templates/images/symbols.svg#favorite"></use></svg>`
- Перед началом разработки нужно запустить команду `gulp`, а перед релизом `gulp release`.