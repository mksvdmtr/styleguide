# RocketScience Styleguide

## Основное

* Будь последователен.
* Не переписывай существующий код чтобы он соответствовал этому стайлгайду.
* Не нарушай стайлгайд без хорошей причины.
* Причина хороша, если ты можешь убедить других что она хороша.

## Язык

"Избегай" значит не делай без хорошей причины.

"Никогда" значит хорошей причины не существует.

## Git

* Не коммитьте мерджи - используйте [rebase workflow] или в простейшем случае [rebase]
* Пишите качественные, внятные [коммит-сообщения].
* Каждый коммит должен содержать время, потраченное на него, в круглых скобках или без них, в самом конце текста (можно на новой строчке, чтобы не засорять лог), в формате (2h) или 5m
* В Git сохраняются UNIX права доступа к файлу. Правильный способ их сбросить в нормальное состояние:
```sh
find . -type d | xargs chmod 0755
find . -type f | xargs chmod 0644
chmod +x bin/*
```

[rebase]: https://github.com/rs-pro/styleguide/wiki/Git-Rebase
[rebase workflow]: http://mettadore.com/analysis/a-simple-git-rebase-workflow-explained/
[коммит-сообщения]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

## Формат (общее)

* Избегай inline комментариев
* Избегай строк длиннее 80 символов.
* Избегай файлов больше 100 строк кода (не считая пустых строк и комментариев).
* Используй SASS @import\@mixin, concerns и т.д.
* Удаляй пробелы в конце всех строк.
* Используй Unix-style line endings (`\n`) ([git eol]).
* Добавляй пустую строку в конце файла [eof]
* Не делай орфографических ошибок, особенно в английских названиях переменных. Если не знаете перевод, посмотрите его [в словаре].
* Не выравнивай символы друг с другом на разных строчках.

```Ruby
# bad
fruits = {
  apple:  1,
  pear:   2,
  banana: 3,
}

# good
fruits = {
  apple: 1,
  pear: 2,
  banana: 3,
}
```

* Если разбиваешь список аргументов, каждый аргумент должен быть на своей строчке, также как и закрывающая скобка.
  
```Ruby
# bad
super_method(arg0, arg1,
  arg2, arg3, arg4)

# good
super_method(
  arg0, 
  arg1,
  arg2, 
  arg3, 
  arg4
)
  ```

* Если разбиваешь хэш, каждый элемент и закрывающая скобка должны быть на своей строчке.
* Используй 2 пробела для оступов (не используй табы).

[git eol]: https://help.github.com/articles/dealing-with-line-endings
[в словаре]: http://slovari.yandex.ru/
[dot guideline example]: https://github.com/thoughtbot/guides/blob/master/style/samples/ruby.rb#L11
[eof]: http://unix.stackexchange.com/questions/23903/should-i-end-my-text-script-files-with-a-newline

## Ruby

* Отделяй многострочные блоки 1 пустой строкой с обоих сторон.
* Use spaces around operators, after commas, colons and semicolons, around { and before }.

```ruby
sum = 1 + 2
a, b = 1, 2
1 > 2 ? true : false; puts "Hi"
[1, 2, 3].each { |e| puts e }
```

* Не добавляй пробелы после `(`, `[` или перед `]`, `)`.

```ruby
some(arg).other
[1, 2, 3].length
```

* Не добавляй пробел после !.

```ruby
!array.include?(element)
```

* Indent when as deep as case.

```ruby
case
when song.name == "Misty"
  puts "Not again!"
when song.duration > 120
  puts "Too long!"
when Time.now.hour > 21
  puts "It's too late"
else
  song.play
end

kind = case year
       when 1850..1889 then "Blues"
       when 1890..1909 then "Ragtime"
       when 1910..1929 then "New Orleans Jazz"
       when 1930..1939 then "Swing"
       when 1940..1950 then "Bebop"
       else "Jazz"
       end
```

* Отделяй методы 1 пустой строкой и чтобы разделить метод на параграфы.

```ruby
def some_method
    data = initialize(options)

    data.manipulate!

    data.result
end

def some_method
    result
end
```

[дополнительно](https://github.com/styleguide/ruby)

## Rails

* Все URL видимые пользователем в адресной строке и индексируемые ПС должны содержать SLUG вместо ID. [в api и внутр. урлах id допустимы]
* В роутах в случае использования ресурсов всегда включай только нужные action'ы
```resources :news, only: [:index, :show]```
* Названия всех моделей и всех полей моделей, видимые в интерфейсе сайта или админке, должны быть переведены на язык сайта
* Перевод моделей и полей моделей должен находиться в config/locales/ru.models.yml

## Прием макета в верстку

Вместе с макетом, должны быть получены следующие вещи:

* ТЗ, хотя бы минимальное
* Шрифты, используемые в макете
* Для всех активных элементов (ссылок, кнопок) должно присутствовать наведенное состояние (очень желательно, но к сожалению, часто отсуствует на практике, поэтому весь макет из за этого пункта мы НЕ заворачиваем)
* Оформление для flash-ей (балуны или инлайновые - в случае если используются только для авторизации в админке, используй стандартное из rocket_cms)
* Оформление ошибок валидации в формах (балуны или инлайновые)
* Минимальный набор элементов форм: input[type=text], textarea, input[type=radio], input[type=checkbox]  - если имеются или планируются на сайте
* Favicon
* select и input[type="file"] обычно также выполняются в стилистике сайта (особенно если другие контролы сильно не похожи на стандартные). Если они нужны, но не показаны в макете, их также требуется получить.

В момент приемки макетов, нужно бегло проверить наличие всех пунктов этого списка в полученных файлах и сообщить о недостающих пунктах.

## CSS

* Используй SASS синтакс
* Используй SCSS синтакс для файлов в css синтаксисе, которые ты не хочешь конвертировать
* Все ссылки на внешние картинки - строго image-url вместо url
* Никогда не используй ```#= require_tree .```
* Избегай более чем трех уровней вложенности селекторов
* Начинай селекторы с класса блока или страницы
* На сайтах с "подвалом" обязательно использовать технику [sticky footer](http://ryanfait.com/sticky-footer/)

### CSS ресет

* Хорошие CSS ресеты:
```css
*
  margin: 0
  padding: 0
```

[normalize](http://necolas.github.io/normalize.css/)

### Организация CSS

Пример хорошей организации CSS:

    stylesheets
    ├── mixins # миксины, переменные специфичные для этого проекта
    │   ├── browser_helpers.css.sass
    │   ├── responsive_helpers.css.sass
    │   └── variables.css.sass
    ├── plugins # сторонние плагины
    │   ├── jquery.fancybox-1.3.4.css
    │   └── reset.css.sass
    ├── pages # CSS отдельных страниц
    │   ├── news.css.sass # для небольших контроллеров (не много css) объедини все экшены в 1 файл
    │   ├── items_show.css.sass
    │   └── items_index.css.sass # разбивай большие контроллеры на отдельные action
    ├── extra # файлы, не включаемые в application.css и загружаемые другим путем
    │   └── editor.css.sass
    ├── blocks # блоки, разделяемые между несколькими страницами
    │   ├── header.css.sass
    │   ├── home-news.css.sass
    │   ├── home-news.css.sass
    │   └── footer.css.sass
    ├── common # общий CSS, не входящий в блоки (формы, текстовый контент и т.д.)
    │   ├── forms.css.sass
    │   ├── text_page.css.sass
    │   └── markdown.css.sass
    ├── application.css.sass
    └── ckcontent.css.sass # CSS для страницы в CKEditor
    
**Весь CSS, использующийся только на одной конкретной странице, должен быть в отдельном файле, соответствующем этой странице. Все селекторы, относящиеся к конкретной странице, должны начинаться с класса ```.#{params[:controller]}_#{params[:action]}```**

SASS\SCSS файлы необходимо всегда загружать через @import, простые CSS файлы - через require. В простом CSS недопустимы ссылки на картинки и другие внешние файлы, кроме случая когда они лежат в папке ```public/```

```sass
#= require_tree ./plugins
#= require my_awesome_styles

@import ../globals/basic

.rule { ... }
```

### Названия классов

Никогда не используй в CSS классы с префиксом ```js-```. ```js-``` только для JS файлов.

Используй префикс ```is-``` для классов состояния которые разделяются между CSS и JS (```is-active```, ```is-hovered```).

## Специфичность (классы vs. ids)

Элементы, которые встречаются на странице всегда строго 1 раз, должны использовать ID, иначе классы. Если сомневаетесь, используйте класс.

Хорошие кандидаты в id: header, footer, уникальные модальные окна.
Плохие: navigation, item listings, item view pages (ex: issue view).

Описание стилей для отдельного блока должно начинаться с класса или идентификатора этого блока. Избегай излишней специфичности селекторов (например, использования наименований тегов совместно с классами):

    <ul class="category-list">
      <li class="item">Category 1</li>
      <li class="item">Category 2</li>
      <li class="item">Category 3</li>
    </ul>

    // namespace блока
    .category-list { 
      li { 
        list-style-type: disc;
      }
      // ссылки хоть и являются вложенными в li, стилизуются одинаково в пределах всего блока
      a { 
        color: #ff0000;
      }
    }

### CSS Specificity guidelines

В пределах одного селектора CSS-идентификатор ```(#selector)``` может встречаться лишь единожды (вначале правила). Пример неправильного оформления: ```#header .search #quicksearch { ... }```.

Когда меняешь существующий элемент для конкретного случая, старайся использовать специфичные имена классов. Вместо ```.listings-layout.bigger``` используй ```.listings-layout.listings-bigger.``` Думай о том как ты будешь позже делать поиск по коду.
The class names disabled, mousedown, danger, hover, selected, and active should always be namespaced by a class (```button.selected``` is a good example).

## HTML

* Используй SLIM. HAML тоже допустим.
* Ставь пробел после =. Это значительно улучшает читаемость кода.

### Партиалы

При верстке, старайся выделять повторяющиеся вещи в партиалы. Хорошие кандидаты в партиал - меню, карточка товара\новости и т.д., любой элемент повторяющийся более чем в одном месте. Также можно выделять в партиалы крупные неповторяющиеся куски кода для улучшения читаемости основной вьюхи.

Элементы, повторяющиеся в трех местах и более обязательно нужно выделять в партиал.

### Организация файлов шаблонов

Пример хорошей организации:

    views
    ├── sections # большие общие разделы страницы (шапка, подвал)
    │   ├── _header.html.slim
    │   └── _footer.html.slim
    ├── items
    │   ├── _show_sidebar.html.slim
    │   ├── _index_sidebar.html.slim
    │   ├── _item_card.html.slim # один товар для списка товаров, может использоваться в разных контроллерах
    │   ├── show # так тоже можно, вместо того что выше и если блоков в show больше 1-2.
    │   │  └── _sidebar.html.slim 
    │   ├── show.html.slim
    │   └── index.html.slim    
    ├── news
    │   ├── _news.html.slim # блок новости, повторяющийся в наскольких шаблонах
    │   ├── index.html.slim
    │   └── show.html.slim
    ├── pages
    │   └── show.html.slim
    └── layouts
        ├── application.html.slim
        ├── print.html.slim
        └── email.html.slim

**Обрати внимание, что пути к блокам во views повторяют пути к блокам в SASS**

**Отдельного контроллера для папки во /views может и не быть. Важно логическое соответствие названия папки и содержимого партиала. Например, карточка товара _card.html.slim помещается в папку /items или /products.**

## JavaScript

### CoffeeScript

* Пиши новый JS на CoffeeScript.
* Используй отступ в два пробела.
* Используй явно скобки ```()``` везде где возможно
* Никогда не используй ```$.get``` или ```$.post```. Вместо этого используй ```$.ajax``` и обязательно укажи обработчик и для ```success``` и для ```error```.
* Используй ```$.fn.on``` вместо ```$.fn.bind```, ```$.fn.delegate``` и ```$.fn.live```.
* Используй ```$ ->``` вместо ```$(document).ready ->```
* Не используй ```;```

## Turbolinks

* Для всех новых проектов используй Turbolinks.

## Готовые плагины / библиотеки

* Если для нужного тебе функционала есть готовый плагин, используй его.
* Если плагин крив и ужасен, не используй его.
* Не правь код готового плагина, если это не баг плагина.
* Если поправил баг в плагине - сделай pull request.
* Если тебе абсолютно необходимо поправить код в самом плагине:
    - Добавь в имя файла плагина слово ```modified```
    - Вверху файла плагина, опиши суть и причину внесенных тобой изменений.
* Никогда не добавляй в проект минифицированный JS (исключение - highslide и аналогичные по сложности библиотеки, находящиеся сразу в папке public).
* Используй библиотеки, уже добавленные в проект. Избегай добавлять библиотеки, сходные по функционалу с уже добавленными в проект.
* Удаляй библиотеки, которые более не используются в проекте.
* Для больших проектов, подлючай библиотеки при помощи Bower, гемов, или другим способом, позволяющим отследить, откуда взята конкретная версия плагина.
* Используй underscore или lodash если в проекте активно используется JS.


## Поддержка броузеров

| Броузер       | Версия    | Mac | Win | *nix |  Коммент               | 
|---------------|-----------|-----|-----|------|------------------------|
| Chrome        | 4-24      | B   | B   |  C   |                        |
| Chrome        | 24-32     | A   | A   |  B   |                        |
| Chrome        | 33        | A   | A+  |  B   |                        |
| Firefox       | 3.5-18    | B   | B   |  C   |                        |
| Firefox       | 19-27     | A   | A   |  B   |                        |
| Firefox       | 28        | A   | A+  |  B   |                        |
| Opera         | 9-10.1    | B   | B   |  C   |                        |
| Opera         | 10.5-12.1 | A   | A   |  C   |                        |
| Opera         | 15-18     | A   | A   |  B   |  Webkit                |
| Opera         | 19        | A   | A+  |  B   |  Webkit                |
| Я.броузер     |           | -   | A   |  -   |  Webkit с кучей багов  |
| Safari        | 5.1       | A   | C   |  -   |  Webkit                |
| Safari        | 6         | A   | C   |  -   |  Webkit                |
| IE            | 6         | -   | -   |  -   |                        |
| IE            | 7         | -   | D   |  -   |                        |
| IE            | 8         | -   | B   |  -   |                        |
| IE            | 9         | -   | A   |  -   |                        |
| IE            | 10        | -   | A+  |  -   |                        |
| IE            | 11        | -   | A   |  -   |                        |

### Легенда

* A+ - Броузер полностью поддерживается. Должен быть тщательно протестирован и идеально работать.
* A  - Броузер поддерживается. Тестируется по мере возможности.
* B  - Броузер поддерживается, но не тестируется. Допустимы незначительные визуальные косяки в верстке.
* С  - Броузер поддерживается частично. Допустимы визуальные косяки, не влияющие на работоспособность.
* D  - Броузер не поддерживается. Основной функционал сайта должен быть минимально работоспособен.
* -  - Броузер не поддерживается.

Для *nix Подразумевается, что установлены шрифты MS (msttcorefonts)

### Поддержка броузеров с отключенным функционалом

Желательно, чтобы если в броузере пользователя выключен минимально необходимый для использования сайта функционал (js, cookies и т.д.) пользователь видел сообщение об ошибке, а не сломанный сайт.

### Поддержка масштабирования страницы пользователем

При масштабировании страницы броузера пользователем, допустимы небольшие визуальные косяки, никак не мешающие работе с сайтом. Недопустима сильно поехавшая из за зума верстка.

## RocketCMS

Все настройки rocket_cms (в т.ч. патчи моделей) должны быть строго в файле ```config/initializers/rocket_cms.rb```

## Прием верстки в программирование

TODO

## Внесение изменений в styleguide

Создай pull request со своим предложением.

## Источники

[thoughtbot styleguide](https://github.com/thoughtbot/guides)

[github styleguide](https://github.com/styleguide)

[ruby style guide](https://github.com/bbatsov/ruby-style-guide)

[rails style guide](https://github.com/bbatsov/rails-style-guide)
