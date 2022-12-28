# wp_star_rating - звездный рейтинг

Оригинальный текст решения находится [здесь](https://wp-kama.ru/function/wp_star_rating).
Выводит HTML разметку со звездами от 0 до ... Понимает половины вроде 4.5 звезды.

## :white_check_mark: Использование

```php
wp_star_rating( $args );
```

$args(массив) - массив аргументов для вывода звезд.

rating(int) - рейтинг который нужно вывести.

Если в type = rating, то число будет считаться рейтингом и будет выведено количество звезд указанных в этом параметре.

Если в type = percent, то число будет считаться процентом и будет показано 5 звезд заполненных в соответствии с указанным числом. По умолчанию: 0

type(string) - формат в котором указан параметр $rating. Может быть: rating или percent. По умолчанию: 'rating'

number(int) - число на основе скольки голосов показан результат, добавить в title атрибут тега. Отставьте 0 чтобы не показывать. По умолчанию: 0

echo(bool) - выводить или возвращать результат? По умолчанию: true

## :white_check_mark: Примеры

```php
wp_star_rating( ['rating'=>7.5, 'type'=>'rating', 'number'=>0 ] );

/* Выведет:
<div class="star-rating" title="Рейтинг 7,5"><span class="screen-reader-text">Рейтинг 7,5</span>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-half"></div>
</div>
*/
```
```php
wp_star_rating( ['rating'=>85, 'type'=>'percent', 'number'=>654 ] );

/* Выведет:
<div class="star-rating" title="Рейтинг 4,5 на основе 654 голосов"><span class="screen-reader-text">Рейтинг 4,5 на основе 654 голосов</span>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-full"></div>
	<div class="star star-half"></div>
</div>
*/
```
## :white_check_mark: Вывод во фронтэнде

Во фронтэнде функция не работает и там лучше сделать свою подобную функцию. Но если у вас подключаются шрифты 'dashicons', то есть смысл использовать эту функцию, для этого нужно подключить нужный файл и css стили:

В файл functions.php:

```php
// для фронта
require_once ABSPATH .'wp-admin/includes/template.php';

// подключим иконки
add_action('wp_enqueue_scripts', function(){    wp_enqueue_style('dashicons');    });
```

В файле где необходимо вывести рейтинг:

```php
wp_star_rating( array( 'rating'=>4.5, 'type'=>'rating', 'number'=>521, ) );
```

CSS:

```css
.screen-reader-text{ position: absolute; margin: -1px; padding: 0; height: 1px; width: 1px; overflow: hidden; clip: rect(0 0 0 0); border: 0; word-wrap: normal!important; }
.star-rating .star-full:before { content: "\f155"; }
.star-rating .star-half:before { content: "\f459"; }
.star-rating .star-empty:before { content: "\f154"; }
.star-rating .star {
	color: #0074A2;
	display: inline-block;
	font-family: dashicons;
	font-size: 20px;
	font-style: normal;
	font-weight: 400;
	height: 20px;
	line-height: 1;
	text-align: center;
	text-decoration: inherit;
	vertical-align: top;
	width: 20px;
}
```
Мой пример с полем ACF:
```php
<div class="testimonial-item-stars">
<?php wp_star_rating( ['rating'=>$testimonial_rating, 'type'=>'rating', 'number'=>0 ] );?>
</div>
```
