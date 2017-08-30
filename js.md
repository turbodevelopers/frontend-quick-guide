## Скрипты

Для организации кода и реализации SPA в проекте используется фреймворк Backbone. Однако совсем не обязательно знать Backbone от и до для того, чтобы начать писать свой js код. Поскольку много полезных фич, таких как, например, роутинг, уже настроены и работают из коробки.

Backbone - MVP фреймворк \([Model-View-Presenter](https://ru.wikipedia.org/wiki/Model-View-Presenter)\), но, как правило, в большинстве проектов не используется Model, а стало быть и Presenter. Работа идет только с [View](http://backbonejs.org/#View), который используется для организации модульности. Отсюда можно воспринимать View просто как модуль.

Во View содержится весь js, который иcпользуется на странице. Таким образом, одна страница = одна вьюха. Вьюха привязывается к странице с помощью атрибута `data-view`. Например, если вы создали страницу `news.php`, то для нее необходимо создать вьюху `News.js`, а на самой странице прописать `data-view="News"`.

```php
// Clean HTML
<div class="news" data-view="News"> ... </div>

// Тоже самое на PHP
<? define('PAGE_JS_VIEW','News'); ?>
<div class="news" data-view="<?=PAGE_JS_VIEW?>"> ... </div>
```

### Структура View

```js
app.ns('app.views').News = app.core.Page.extend({

    events: {},                                                       // Обработчики событий

    initialize: function() {                                          // Инициализация вьюхи
        app.views.News.__super__.initialize.apply(this, arguments); 
    },

    remove: function() {                                              // Удаление вьюхи и обработчиков
        app.views.News.__super__.remove.apply(this, arguments); 
    },

    render: function() {                                              // Отрисовка разметки
        app.views.News.__super__.render.apply(this, arguments);
        app.views.News.__super__.afterRender.apply(this, arguments);
    }

});
```

### Работа с View

Свой код нужно писать в методе `render()`.

Обработчики событий нужно вешать декларативно в объекте `events` \(это стандартное [делегирование событий в Backbone](http://backbonejs.org/#View-delegateEvents)\). События записываются в следующем формате `{"событие селектор": "обработчик"}`. Например:

```js
events: {
  'click .js-filter-reset': 'e_resetFilters',
  'change .a-checkbox__input': 'e_toggleCheckbox',
  'keyup .js-search-input': '_e_searchInput',
  'focus .js-search-input': function () { ... },
},
```

Профит от такого подхода в том, что при уходе со страницы \(при смене вьюхи\) обработчики снимаются автоматически.

**Обратите внимание \#1!** Backbone требует, чтобы вьюхи были привязаны к конкретному DOM элементу. По-умолчанию таким элементом является `<div class="grid"></div>`. Поэтому если в верстке вы по какой-то причине решили изменить класс корневого элемента для вьюх, не забудьте поменять его также и в `Application.js`!

**Обратите внимание \#2!** Если по какой-то причине вы вешаете обработчик jQuery способом, то нужно обязательно его снять в методе `remove()`. Иначе при уходе на другую страницу обработчик так и останется висеть в памяти, что грозит ее утечкой. Чем больше неиспользуемых обработчиков в памяти, тем серьезней утечка и медленнее работает сайт. Это не касается вьюх, чей код используется на всем сайте \(`Header.js`, `Footer.js` и т.п.\).

### Работа с subView

Код, который используется на нескольких страницах, нужно класть в папку `subView` и вызывать на тех страницах, где необходимо. Работа с сабвьюхами почти ничем не отличается от работы с вьюхами за исключением того, что для сабвьюх всегда нужно указывать корневой DOM элемент в свойстве `el`.

```js
app.views.MarkNewsAsRead = Backbone.View.extend({

  el: '.article',

  ...

});
```

Вызов сабвьюхи выглядит следующим образом:

```js
this.subView['MarkNewsAsRead'] = new app.views.MarkNewsAsRead();
this.subView['MarkNewsAsRead'].render();

// или так
var MarkNewsAsRead = this.subView['MarkNewsAsRead'] = new app.views.MarkNewsAsRead();
MarkNewsAsRead.render();
```


